# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-23T14:20:01.555796+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×41 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×57 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×41 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×34  [2026-07-23T14:03:36]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×34  [2026-07-23T14:03:36]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-07-23T14:03:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×43  [2026-07-23T13:37:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×45  [2026-07-23T13:35:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-23T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-23T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×4  [2026-07-23T10:57:27]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ORPHAN_SCAN  ×1  [2026-07-23T06:00:07]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-23T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2268 actual=0.2667 gap=-0.0399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-23T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1798 actual=0.4286 gap=-0.2488`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-23T06:00:07]
- key: `ROI_STAT|S00: n=179 hit%=27.4% hit_CI[Bonf]=[18.9,37.8]% ROI=0.72 ROI_boot95=[0.53,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-23T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-23T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=29.4% hit_CI[Bonf]=[20.3,40.6]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-23T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-23T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=71 hit%=47.9% hit_CI[Bonf]=[31.9,64.3]% ROI=0.96 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-23T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-23T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=25.8% ROI=0.57 (コスト 9,100/回収 5,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-23T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.89 (コスト 11,200/回収 9,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-23T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=79 hit%=35.4% ROI=0.85 (コスト 18,100/回収 15,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.44MB / last modified 2026-07-23T14:19:03.744510+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
FO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-23 14:17:04,271 [INFO] predictor: Models loaded OK
2026-07-23 14:17:04,468 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-23 14:18:03,739 [INFO] run_cycle: === run_cycle 14:18:03 ===
2026-07-23 14:18:03,739 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-23 14:18:03,739 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-23 14:18:03,767 [INFO] predictor: Models loaded OK
2026-07-23 14:18:15,279 [INFO] scraper: odds3t: 120/120 parsed
2026-07-23 14:18:16,409 [INFO] scraper: odds3f: 20/20 parsed
2026-07-23 14:18:17,495 [INFO] scraper: odds2t: 30/30 parsed
2026-07-23 14:18:17,496 [INFO] scraper: odds2f: 15/15 parsed
2026-07-23 14:18:18,597 [INFO] scraper: odds_win: 6/6 parsed
2026-07-23 14:18:18,597 [INFO] scraper: fetch_race 03/8: boats=6 odds=191/191
2026-07-23 14:18:18,601 [INFO] predictor: CALIBRATION_MODE=on
2026-07-23 14:18:18,601 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-23 14:18:18,604 [INFO] run_cycle: fetched 03/8 [scan]: 156 combos
2026-07-23 14:18:18,805 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-23 14:19:03,349 [INFO] run_cycle: === run_cycle 14:19:03 ===
2026-07-23 14:19:03,349 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-23 14:19:03,349 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-23 14:19:03,391 [INFO] predictor: Models loaded OK
2026-07-23 14:19:03,556 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-23 14:20:04,840 [INFO] run_cycle: === run_cycle 14:20:04 ===
2026-07-23 14:20:04,840 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-23 14:20:04,840 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-23 14:20:04,891 [INFO] predictor: Models loaded OK

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 11, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 165
  FINAL_MISSING: 57
  CIRCUIT_BREAKER_TRIP: 41
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 26
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 9 | 12,900 | 7,890 | -5,010 | 0.612 |
| S01_NAKAANA1 | 40 | 6 | 8,000 | 4,480 | -3,520 | 0.56 |
| S02_TETSUBAN | 20 | 11 | 4,000 | 4,180 | +180 | 1.045 |

## 直近アラート (24h・新しい順)
```
[14:19:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1076}
[14:16:43] FINAL_MISSING: {"deadline": "2026-07-23T10:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072321061045", "sid": "S00"}
[14:16:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1098}
[14:15:26] FINAL_MISSING: {"deadline": "2026-07-23T13:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072322041345", "sid": "S00"}
[14:12:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1132}
[14:09:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1104}
[14:08:44] FINAL_MISSING: {"deadline": "2026-07-23T12:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072309051238", "sid": "S00"}
[14:07:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1113}
[14:06:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1118}
[14:05:25] FINAL_MISSING: {"deadline": "2026-07-23T13:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072314111335", "sid": "S00"}
```

## 本日残レース: 78件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 78件 締切済
- 通知発射: scan=18 nid / final=15 nid / result=8 nid
- predictions: 9 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 14:01:29 |
| S02_TETSUBAN | 097R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 13:36:29 |
| S02_TETSUBAN | 054R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.2 drift=+4.5% | 13:00:27 |
| S00 | 2310R | win | 1 | 0.4111 | 5.4 | 2.22 | 300 | scan=14.2 drift=-62.0% | 12:53:19 |
| S00 | 149R | win | 1 | 0.5735 | 12.1 | 6.94 | 300 | scan=6.7 drift=+80.6% | 12:24:19 |
| S00 | 032R | win | 1 | 0.1371 | 5.5 | 0.75 | 300 | scan=4.7 drift=+17.0% | 11:38:19 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5891 | 3.9 | 2.30 | 200 | scan=4.2 drift=-7.1% | 11:19:20 |
| S02_TETSUBAN | 092R | win | 1 | 0.5719 | 2.3 | 1.32 | 200 | scan=- drift=- | 11:01:20 |
| S02_TETSUBAN | 213R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 09:21:18 |
| S01_NAKAANA1 | 246R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 19:53:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +21.8% | -83.7% | +628.9% | 20 | 9 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 506.7s |
| **Latency** (scan→final max) | 618.7s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 413 | 0.4699 | 0.3148 | +0.1551 | 🟡+33% | 0.2363 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4301 | 0.2768 | 0.2284 | 🔴-0.14 | 0.728 |
| S01_NAKAANA1 | win | 161 | 0.4793 | 0.2795 | 0.2374 | 🔴-0.18 | 0.765 |
| S02_TETSUBAN | win | 75 | 0.5436 | 0.4800 | 0.2525 | 🔴-0.01 | 0.953 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1313 | 0.2000 | 🔴-0.0687 |
| 0.15-0.20 | 6 | 0.1804 | 0.5000 | 🔴-0.3196 |
| 0.20-0.30 | 14 | 0.2266 | 0.2857 | 🔴-0.0591 |
| 0.30-0.50 | 160 | 0.4172 | 0.2687 | 🔴+0.1484 |
| 0.50+ | 225 | 0.5429 | 0.3511 | 🔴+0.1918 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 82 | 0.81 |
| win | <5.0 | ✅learned | 150 | 0.722 |
| win | <10.0 | ✅learned | 77 | 0.461 |
| win | <20.0 | ✅learned | 25 | 0.218 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-07-23T14:20:01.555796+09:00_