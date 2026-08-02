# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-02T11:20:01.959763+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🟡 FINAL_MISSING×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-08-02T11:03:31]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×17  [2026-08-02T11:03:31]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-08-02T11:03:31]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-08-02T10:54:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×44  [2026-08-02T10:00:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-02T10:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×19  [2026-08-02T09:29:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-02T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-02T06:00:10]
- key: `ORPHAN_SCAN|169 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-02T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-02T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-02T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1785 actual=0.3750 gap=-0.1965`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-02T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=35.9% ROI=0.87 (コスト 9,600/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-02T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2289 actual=0.3333 gap=-0.1044`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-02T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=31 pred=0.3238 actual=0.1613 gap=+0.1625`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-02T06:00:10]
- key: `ROI_STAT|S00: n=178 hit%=27.5% hit_CI[Bonf]=[19.0,38.0]% ROI=0.74 ROI_boot95=[0.54,0.99]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-02T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=165 hit%=26.1% hit_CI[Bonf]=[17.5,36.9]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-02T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=52.5% hit_CI[Bonf]=[36.9,67.6]% ROI=1.03 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-02T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=28.1% ROI=0.67 (コスト 9,400/回収 6,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-02T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=73 hit%=31.5% ROI=0.74 (コスト 16,900/回収 12,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.22MB / last modified 2026-08-02T11:19:55.387842+09:00

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
 11:19:15,063 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260802: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-02 11:19:26,091 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260802: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-08-02 11:19:39,123 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260802: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-08-02 11:19:39,124 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260802
2026-08-02 11:19:39,124 [ERROR] scraper: racelist fetch failed: jcd=13 rno=3
2026-08-02 11:19:39,124 [WARNING] run_cycle: fetch None: 13/3
2026-08-02 11:19:51,608 [INFO] scraper: odds3t: 120/120 parsed
2026-08-02 11:19:52,713 [INFO] scraper: odds3f: 20/20 parsed
2026-08-02 11:19:53,799 [INFO] scraper: odds2t: 30/30 parsed
2026-08-02 11:19:53,800 [INFO] scraper: odds2f: 15/15 parsed
2026-08-02 11:19:54,878 [INFO] scraper: odds_win: 6/6 parsed
2026-08-02 11:19:54,878 [INFO] scraper: fetch_race 05/1: boats=6 odds=191/191
2026-08-02 11:19:54,881 [INFO] predictor: CALIBRATION_MODE=on
2026-08-02 11:19:54,881 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-02 11:19:54,885 [INFO] run_cycle: fetched 05/1 [scan]: 156 combos
2026-08-02 11:19:55,005 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-02 11:20:05,187 [INFO] run_cycle: === run_cycle 11:20:05 ===
2026-08-02 11:20:05,187 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-02 11:20:05,187 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-02 11:20:05,253 [INFO] predictor: Models loaded OK

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
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 14, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 117
  CIRCUIT_BREAKER_NO_ACTION: 29
  CIRCUIT_BREAKER_TRIP: 26
  FINAL_MISSING: 26
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 8 | 10,800 | 6,510 | -4,290 | 0.603 |
| S01_NAKAANA1 | 38 | 12 | 7,600 | 7,420 | -180 | 0.976 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 1,920 | -1,480 | 0.565 |

## 直近アラート (24h・新しい順)
```
[11:04:42] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 6510, "roi_7d": 0.603, "sid": "S00"}
[11:03:30] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:03:30] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6510, "roi_7d": 0.62, "sid": "S00"}
[11:03:30] FINAL_MISSING: {"deadline": "2026-08-02T08:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080221010832", "sid": "S00"}
[11:03:30] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:54:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.493, "baseline_mean": 0.826, "baseline_stdev": 0.105, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -4.68}
[10:02:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:02:04] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6510, "roi_7d": 0.62, "sid": "S00"}
[10:02:04] FINAL_MISSING: {"deadline": "2026-08-02T08:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080221010832", "sid": "S00"}
[10:02:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 125件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 19件 締切済
- 通知発射: scan=3 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 082R | win | 1 | 0.4989 | 6.9 | 3.44 | 300 | scan=5.2 drift=+32.7% | 11:04:30 |
| S01_NAKAANA1 | 216R | win | 1 | 0.5123 | 4.6 | 2.36 | 200 | scan=- drift=- | 10:44:19 |
| S01_NAKAANA1 | 156R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 17:55:43 |
| S01_NAKAANA1 | 069R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.1 drift=+6.5% | 15:33:19 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5334 | 4.1 | 2.19 | 200 | scan=3.1 drift=+32.3% | 15:25:20 |
| S00 | 226R | win | 1 | 0.5174 | 4.8 | 2.48 | 300 | scan=10.1 drift=-52.5% | 14:53:19 |
| S01_NAKAANA1 | 067R | win | 1 | 0.5544 | 4.7 | 2.61 | 200 | scan=- drift=- | 14:25:19 |
| S01_NAKAANA1 | 136R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=3.3 drift=+6.1% | 13:00:30 |
| S00 | 163R | win | 1 | 0.5174 | 24.0 | 12.42 | 300 | scan=- drift=- | 12:55:19 |
| S00 | 085R | win | 1 | 0.1084 | 16.6 | 1.80 | 300 | scan=12.1 drift=+37.2% | 12:37:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +17.3% | -65.9% | +375.6% | 14 | 8 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 505.2s |
| **Latency** (scan→final max) | 670.1s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 422 | 0.4616 | 0.3152 | +0.1464 | 🟡+32% | 0.2356 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4204 | 0.2753 | 0.2312 | 🔴-0.16 | 0.744 |
| S01_NAKAANA1 | win | 165 | 0.4731 | 0.2606 | 0.2349 | 🔴-0.22 | 0.78 |
| S02_TETSUBAN | win | 79 | 0.5301 | 0.5190 | 0.2467 | ✅+0.01 | 1.01 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1241 | 0.2000 | 🔴-0.0759 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 12 | 0.2289 | 0.3333 | 🔴-0.1044 |
| 0.30-0.50 | 167 | 0.4173 | 0.2575 | 🔴+0.1598 |
| 0.50+ | 221 | 0.5399 | 0.3665 | 🔴+0.1734 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 91 | 0.796 |
| win | <5.0 | ✅learned | 166 | 0.724 |
| win | <10.0 | ✅learned | 86 | 0.455 |
| win | <20.0 | ✅learned | 27 | 0.218 |
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
_auto-generated by claude_snapshot.py at 2026-08-02T11:20:01.959763+09:00_