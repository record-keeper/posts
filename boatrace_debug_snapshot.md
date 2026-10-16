# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-16T09:50:02.399828+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×1 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-16T09:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×49  [2026-10-16T09:01:10]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×49  [2026-10-16T09:01:10]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ORPHAN_SCAN  ×1  [2026-10-16T06:00:19]
- key: `ORPHAN_SCAN|156 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=87<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=180<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S00: n=180 hit%=26.7% hit_CI[Bonf]=[18.3,37.1]% ROI=0.73 ROI_boot95=[0.53,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=170 hit%=35.3% hit_CI[Bonf]=[25.6,46.3]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=87 hit%=51.7% hit_CI[Bonf]=[36.8,66.3]% ROI=0.93 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=39.4% ROI=1.00 (コスト 9,500/回収 9,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=32.0% ROI=0.74 (コスト 11,800/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=38.5% ROI=1.09 (コスト 21,000/回収 22,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=58 hit%=36.2% ROI=0.86 (コスト 13,800/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=23.9% ROI=0.79 (コスト 11,800/回収 9,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=437 pred=0.4784 actual=0.3501 error=+0.1283 (+27%) brier=0.2482 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=180 pred=0.4435 hit=0.2667 cal_err=+0.1768 brier=0.2458 BSS=-0.26 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=170 pred=0.4898 hit=0.3529 cal_err=+0.1369 brier=0.2450 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=87 pred=0.5283 hit=0.5172 cal_err=+0.0111 brier=0.2594 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1249 actual=0.4000 gap=-0.2751`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.88MB / last modified 2026-10-16T09:49:06.306646+09:00

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
t=5000
2026-10-16 09:48:05,106 [INFO] predictor: Models loaded OK
2026-10-16 09:48:16,157 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=14&hd=20261016: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-16 09:48:27,548 [INFO] scraper: odds3t: 120/120 parsed
2026-10-16 09:48:28,672 [INFO] scraper: odds3f: 20/20 parsed
2026-10-16 09:48:29,769 [INFO] scraper: odds2t: 30/30 parsed
2026-10-16 09:48:29,771 [INFO] scraper: odds2f: 15/15 parsed
2026-10-16 09:48:30,870 [INFO] scraper: odds_win: 6/6 parsed
2026-10-16 09:48:30,870 [INFO] scraper: fetch_race 14/4: boats=6 odds=191/191
2026-10-16 09:48:30,874 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 09:48:30,874 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-16 09:48:30,878 [INFO] run_cycle: fetched 14/4 [scan]: 156 combos
2026-10-16 09:48:34,397 [INFO] scraper: odds3t: 120/120 parsed
2026-10-16 09:48:36,067 [INFO] scraper: odds3f: 20/20 parsed
2026-10-16 09:48:37,151 [INFO] scraper: odds2t: 28/30 parsed
2026-10-16 09:48:37,152 [INFO] scraper: odds2f: 12/15 parsed
2026-10-16 09:48:38,232 [INFO] scraper: odds_win: 3/6 parsed
2026-10-16 09:48:38,232 [INFO] scraper: fetch_race 21/4: boats=6 odds=183/191
2026-10-16 09:48:38,235 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 09:48:38,235 [INFO] predictor: combos: {'win': 3, '2t': 28, '3t': 120}
2026-10-16 09:48:38,239 [INFO] run_cycle: fetched 21/4 [scan]: 151 combos
2026-10-16 09:48:38,405 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-16 09:49:04,682 [INFO] run_cycle: === run_cycle 09:49:04 ===
2026-10-16 09:49:04,682 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-16 09:49:04,682 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-16 09:49:04,728 [INFO] predictor: Models loaded OK
2026-10-16 09:49:04,917 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 19, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 118
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 14
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_SPIKE: 3
  CIRCUIT_BREAKER_TRIP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 11 | 13,500 | 11,220 | -2,280 | 0.831 |
| S01_NAKAANA1 | 41 | 16 | 8,200 | 6,200 | -2,000 | 0.756 |
| S02_TETSUBAN | 21 | 12 | 4,200 | 4,300 | +100 | 1.024 |

## 直近アラート (24h・新しい順)
```
[09:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[08:00:53] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:53] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:56:04] FINAL_MISSING: {"deadline": "2026-10-15T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101502021116", "sid": "S00"}
[23:47:06] FINAL_MISSING: {"deadline": "2026-10-15T17:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101524051715", "sid": "S00"}
[23:36:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 147件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 9件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 248R | win | 1 | 0.1156 | 5.4 | 0.62 | 300 | scan=4.8 drift=+12.5% | 18:36:20 |
| S01_NAKAANA1 | 244R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=- drift=- | 16:46:19 |
| S00 | 153R | win | 1 | 0.5735 | 5.2 | 2.98 | 300 | scan=5.2 drift=+0.0% | 16:10:31 |
| S00 | 2211R | win | 1 | 0.2290 | 8.1 | 1.85 | 300 | scan=- drift=- | 16:04:18 |
| S00 | 242R | win | 1 | 0.3177 | 5.2 | 1.65 | 300 | scan=4.5 drift=+15.6% | 15:44:20 |
| S01_NAKAANA1 | 029R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.5 drift=-31.1% | 14:43:22 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.2 drift=+18.2% | 14:36:30 |
| S00 | 028R | win | 1 | 0.3599 | 7.8 | 2.81 | 300 | scan=13.5 drift=-42.2% | 14:12:19 |
| S01_NAKAANA1 | 1411R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=3.0 drift=+10.0% | 13:31:19 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.7 drift=-5.4% | 12:55:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 68 | +16.4% | -52.2% | +326.7% | 16 | 7 | 47 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 392.5s |
| **Latency** (scan→final max) | 593.5s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4784 | 0.3501 | +0.1283 | 🟡+27% | 0.2482 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4435 | 0.2667 | 0.2458 | 🔴-0.26 | 0.734 |
| S01_NAKAANA1 | win | 170 | 0.4898 | 0.3529 | 0.2450 | 🔴-0.07 | 1.014 |
| S02_TETSUBAN | win | 87 | 0.5283 | 0.5172 | 0.2594 | 🔴-0.04 | 0.925 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1249 | 0.4000 | 🔴-0.2751 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 162 | 0.4173 | 0.3148 | 🔴+0.1025 |
| 0.50+ | 255 | 0.5430 | 0.3765 | 🔴+0.1665 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 183 | 0.772 |
| win | <5.0 | ✅learned | 327 | 0.75 |
| win | <10.0 | ✅learned | 142 | 0.463 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-16T09:50:02.399828+09:00_