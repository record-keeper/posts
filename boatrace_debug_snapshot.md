# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-02T13:30:02.502821+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×71 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-10-02T13:23:23]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×24  [2026-10-02T13:05:46]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×24  [2026-10-02T13:05:46]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×24  [2026-10-02T13:05:46]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-02T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-10-02T12:20:53]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-10-02T11:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×59  [2026-10-02T10:56:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ORPHAN_SCAN  ×1  [2026-10-02T06:00:26]
- key: `ORPHAN_SCAN|182 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-02T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-02T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-02T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=159<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-02T06:00:26]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-02T06:00:26]
- key: `ROI_STAT|S00: n=169 hit%=21.3% hit_CI[Bonf]=[13.7,31.6]% ROI=0.61 ROI_boot95=[0.41,0.84]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-02T06:00:26]
- key: `ROI_STAT|S01_NAKAANA1: n=159 hit%=25.8% hit_CI[Bonf]=[17.2,36.8]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-02T06:00:26]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=48.8% hit_CI[Bonf]=[33.5,64.2]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=35.5% ROI=1.00 (コスト 8,700/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=24.4% ROI=0.65 (コスト 10,500/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=26.7% ROI=0.79 (コスト 20,900/回収 16,520)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-02T06:00:26]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=43 hit%=27.9% ROI=0.50 (コスト 9,700/回収 4,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.78MB / last modified 2026-10-02T13:29:52.237554+09:00

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
mbos: {'win': 6, '2t': 30, '3t': 120}
2026-10-02 13:29:21,163 [INFO] run_cycle: fetched 04/6 [final]: 156 combos
2026-10-02 13:29:24,879 [INFO] scraper: odds3t: 120/120 parsed
2026-10-02 13:29:25,970 [INFO] scraper: odds3f: 20/20 parsed
2026-10-02 13:29:27,196 [INFO] scraper: odds2t: 30/30 parsed
2026-10-02 13:29:27,198 [INFO] scraper: odds2f: 15/15 parsed
2026-10-02 13:29:28,351 [INFO] scraper: odds_win: 6/6 parsed
2026-10-02 13:29:28,351 [INFO] scraper: fetch_race 14/11: boats=6 odds=191/191
2026-10-02 13:29:28,353 [INFO] predictor: CALIBRATION_MODE=on
2026-10-02 13:29:28,354 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-02 13:29:28,357 [INFO] run_cycle: fetched 14/11 [scan]: 156 combos
2026-10-02 13:29:32,175 [INFO] scraper: odds3t: 120/120 parsed
2026-10-02 13:29:34,437 [INFO] scraper: odds3f: 19/20 parsed
2026-10-02 13:29:35,577 [INFO] scraper: odds2t: 30/30 parsed
2026-10-02 13:29:35,579 [INFO] scraper: odds2f: 15/15 parsed
2026-10-02 13:29:36,692 [INFO] scraper: odds_win: 4/6 parsed
2026-10-02 13:29:36,692 [INFO] scraper: fetch_race 22/6: boats=6 odds=188/191
2026-10-02 13:29:36,695 [INFO] predictor: CALIBRATION_MODE=on
2026-10-02 13:29:36,695 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-02 13:29:36,699 [INFO] run_cycle: fetched 22/6 [scan]: 154 combos
2026-10-02 13:29:40,359 [INFO] scraper: odds3t: 120/120 parsed
2026-10-02 13:29:41,493 [INFO] scraper: odds3f: 19/20 parsed
2026-10-02 13:29:42,609 [INFO] scraper: odds2t: 29/30 parsed
2026-10-02 13:29:42,610 [INFO] scraper: odds2f: 15/15 parsed
2026-10-02 13:29:43,716 [INFO] scraper: odds_win: 6/6 parsed
2026-10-02 13:29:43,716 [INFO] scraper: fetch_race 23/11: boats=6 odds=189/191
2026-10-02 13:29:43,719 [INFO] predictor: CALIBRATION_MODE=on
2026-10-02 13:29:43,719 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-10-02 13:29:43,723 [INFO] run_cycle: fetched 23/11 [scan]: 155 combos
2026-10-02 13:29:43,892 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 81
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 81
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 22, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 121
  FINAL_MISSING: 71
  CIRCUIT_BREAKER_NO_ACTION: 27
  CIRCUIT_BREAKER_TRIP: 26
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 10 | 13,800 | 7,830 | -5,970 | 0.567 |
| S01_NAKAANA1 | 47 | 13 | 9,400 | 8,340 | -1,060 | 0.887 |
| S02_TETSUBAN | 19 | 11 | 3,800 | 3,760 | -40 | 0.989 |

## 直近アラート (24h・新しい順)
```
[13:26:34] FINAL_MISSING: {"deadline": "2026-10-02T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100204031155", "sid": "S00"}
[13:23:23] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.128, "baseline_mean": 0.795, "baseline_stdev": 0.057, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 9, "z_score": -2.23}
[13:05:40] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:05:40] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:53:28] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 7830, "roi_7d": 0.567, "sid": "S00"}
[12:41:40] FINAL_MISSING: {"deadline": "2026-10-02T09:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100223020909", "sid": "S00"}
[12:36:21] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 7830, "roi_7d": 0.555, "sid": "S00"}
[12:25:22] FINAL_MISSING: {"deadline": "2026-10-02T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100204031155", "sid": "S00"}
[12:20:52] SEND_WITHOUT_DBREC: {"kind": "SEND_WITHOUT_DBREC", "nid": "2026100214081148", "phase": "result", "sid": "S01_NAKAANA1"}
[12:17:56] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 18.7, "final": 3.8, "kind": "LARGE_ODDS_DRIFT", "race": "063R", "scan": 3.2, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 103件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 65件 締切済
- 通知発射: scan=9 nid / final=11 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 239R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=- drift=- | 12:33:19 |
| S01_NAKAANA1 | 063R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=3.2 drift=+18.7% | 12:17:31 |
| S00 | 223R | win | 1 | 0.5735 | 9.0 | 5.16 | 300 | scan=6.0 drift=+50.0% | 12:04:19 |
| S01_NAKAANA1 | 062R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=3.1 drift=+6.5% | 11:49:19 |
| S01_NAKAANA1 | 148R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:45:45 |
| S00 | 187R | win | 1 | 0.5334 | 4.7 | 2.51 | 300 | scan=- drift=- | 11:35:20 |
| S00 | 222R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=6.0 drift=-5.0% | 11:33:20 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=- drift=- | 10:52:20 |
| S01_NAKAANA1 | 234R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=- drift=- | 09:58:21 |
| S00 | 197R | win | 1 | 0.2267 | 6.0 | 1.36 | 300 | scan=4.5 drift=+33.3% | 18:12:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 73 | +7.8% | -76.2% | +357.1% | 24 | 10 | 52 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 460.1s |
| **Latency** (scan→final max) | 662.0s |
| **Traffic** (notifications 24h) | 81 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 411 | 0.4781 | 0.2871 | +0.1910 | 🟡+40% | 0.2451 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4461 | 0.2202 | 0.2412 | 🔴-0.40 | 0.639 |
| S01_NAKAANA1 | win | 163 | 0.4892 | 0.2577 | 0.2452 | 🔴-0.28 | 0.803 |
| S02_TETSUBAN | win | 80 | 0.5227 | 0.4875 | 0.2532 | 🔴-0.01 | 0.825 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 157 | 0.4160 | 0.2293 | 🔴+0.1867 |
| 0.50+ | 238 | 0.5424 | 0.3277 | 🔴+0.2146 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 165 | 0.77 |
| win | <5.0 | ✅learned | 284 | 0.759 |
| win | <10.0 | ✅learned | 131 | 0.461 |
| win | <20.0 | ✅learned | 34 | 0.237 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-10-02T13:30:02.502821+09:00_