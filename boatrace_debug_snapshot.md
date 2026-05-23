# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-23T13:00:02.063033+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-05-23T12:02:46]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×58  [2026-05-23T12:02:46]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-05-23T11:10:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×43  [2026-05-23T10:00:10]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-05-23T06:00:10]
- key: `ORPHAN_SCAN|240 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1288 actual=0.2000 gap=-0.0712`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S00: n=196 hit%=28.6% hit_CI[Bonf]=[20.3,38.6]% ROI=0.96 ROI_boot95=[0.71,1.24]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=196<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=65 hit%=32.3% hit_CI[Bonf]=[18.4,50.2]% ROI=0.85 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-23T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=45.0% hit_CI[Bonf]=[25.2,66.5]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-23T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=50 hit%=32.0% ROI=0.86 (コスト 14,800/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=30.8% ROI=1.28 (コスト 9,300/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=59 hit%=27.1% ROI=0.92 (コスト 14,400/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=23 hit%=34.8% ROI=1.31 (コスト 5,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-23T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=18.4% ROI=0.51 (コスト 10,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=301 pred=0.4570 actual=0.3156 error=+0.1414 (+31%) brier=0.2332 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-23T06:00:10]
- key: `CALIBRATION_LIVE|S00(win): n=196 pred=0.4369 hit=0.2857 cal_err=+0.1512 brier=0.2267 BSS=-0.11 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.22MB / last modified 2026-05-23T13:00:04.985008+09:00

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
:05,704 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-23 12:59:05,830 [INFO] run_cycle: === run_cycle 12:59:05 ===
2026-05-23 12:59:05,830 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-23 12:59:05,830 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-23 12:59:05,874 [INFO] predictor: Models loaded OK
2026-05-23 12:59:18,292 [INFO] scraper: odds3t: 120/120 parsed
2026-05-23 12:59:19,422 [INFO] scraper: odds3f: 20/20 parsed
2026-05-23 12:59:20,523 [INFO] scraper: odds2t: 30/30 parsed
2026-05-23 12:59:20,524 [INFO] scraper: odds2f: 15/15 parsed
2026-05-23 12:59:21,627 [INFO] scraper: odds_win: 5/6 parsed
2026-05-23 12:59:21,627 [INFO] scraper: fetch_race 09/6: boats=6 odds=190/191
2026-05-23 12:59:21,640 [INFO] predictor: CALIBRATION_MODE=on
2026-05-23 12:59:21,640 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-23 12:59:21,648 [INFO] run_cycle: fetched 09/6 [final]: 155 combos
2026-05-23 12:59:22,744 [INFO] race_id: notif: nid=2026052309061302 sid=S01_NAKAANA1 phase=final rank=B
2026-05-23 12:59:23,205 [INFO] notifier: Discord notify OK (status=204)
2026-05-23 12:59:24,139 [INFO] notifier: Discord notify OK (status=204)
2026-05-23 12:59:24,311 [INFO] run_cycle: FINAL S01_NAKAANA1 津6R B
2026-05-23 12:59:27,770 [INFO] scraper: odds3t: 120/120 parsed
2026-05-23 12:59:28,910 [INFO] scraper: odds3f: 20/20 parsed
2026-05-23 12:59:30,030 [INFO] scraper: odds2t: 30/30 parsed
2026-05-23 12:59:30,031 [INFO] scraper: odds2f: 15/15 parsed
2026-05-23 12:59:31,097 [INFO] scraper: odds_win: 6/6 parsed
2026-05-23 12:59:31,097 [INFO] scraper: fetch_race 18/10: boats=6 odds=191/191
2026-05-23 12:59:31,107 [INFO] predictor: CALIBRATION_MODE=on
2026-05-23 12:59:31,107 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-23 12:59:31,115 [INFO] run_cycle: fetched 18/10 [scan]: 156 combos
2026-05-23 12:59:31,215 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 15, 'scan': 20}

## アラート件数 (24h・種類別)
```
  KS_ODDS_DRIFT: 35
  ANOMALY_SCRAPER_FAILURE_BURST: 29
  FINAL_MISSING: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 9
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 3
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 14 | 9,600 | 16,020 | +6,420 | 1.669 |
| S01_NAKAANA1 | 27 | 7 | 5,400 | 5,420 | +20 | 1.004 |
| S02_TETSUBAN | 15 | 5 | 3,000 | 1,640 | -1,360 | 0.547 |

## 直近アラート (24h・新しい順)
```
[12:59:31] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001379, "ks_stat": 0.25}
[12:41:47] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001931, "ks_stat": 0.246}
[12:24:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002697, "ks_stat": 0.241}
[12:02:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:59:35] FINAL_MISSING: {"deadline": "2026-05-23T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052309031129", "sid": "S00"}
[11:54:41] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001684, "ks_stat": 0.248}
[11:54:41] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 28.6, "final": 2.7, "kind": "LARGE_ODDS_DRIFT", "race": "114R", "scan": 2.1, "sid": "S02_TETSUBAN"}
[11:50:50] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002381, "ks_stat": 0.243}
[11:50:50] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.206, "baseline_mean": 0.831, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 8, "z_score": -1.89}
[11:47:44] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.331, "baseline_mean": 0.831, "baseline_stdev": 0.109, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 8, "z_score": -3.04}
```

## 本日残レース: 97件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 59件 締切済
- 通知発射: scan=10 nid / final=11 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=- drift=- | 12:59:21 |
| S02_TETSUBAN | 053R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 12:41:46 |
| S02_TETSUBAN | 114R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=2.1 drift=+28.6% | 11:54:32 |
| S01_NAKAANA1 | 108R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=4.9 drift=-28.6% | 11:50:35 |
| S00 | 237R | win | 1 | 0.4989 | 4.5 | 2.25 | 300 | scan=6.0 drift=-25.0% | 11:12:21 |
| S00 | 236R | win | 1 | 0.3177 | 6.2 | 1.97 | 300 | scan=6.0 drift=+3.3% | 10:43:21 |
| S01_NAKAANA1 | 197R | win | 1 | 0.5998 | 3.4 | 2.04 | 200 | scan=3.5 drift=-2.9% | 20:22:22 |
| S00 | 019R | win | 1 | 0.4111 | 5.2 | 2.14 | 300 | scan=11.0 drift=-52.7% | 19:10:35 |
| S01_NAKAANA1 | 015R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=3.2 drift=+31.2% | 17:23:45 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=- drift=- | 16:59:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 43 | +2.4% | -74.9% | +148.9% | 16 | 8 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 415.8s |
| **Latency** (scan→final max) | 638.4s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 305 | 0.4569 | 0.3148 | +0.1422 | 🟡+31% | 0.2342 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 198 | 0.4366 | 0.2879 | 0.2281 | 🔴-0.11 | 0.968 |
| S01_NAKAANA1 | win | 66 | 0.4848 | 0.3182 | 0.2421 | 🔴-0.12 | 0.836 |
| S02_TETSUBAN | win | 41 | 0.5101 | 0.4390 | 0.2508 | 🔴-0.02 | 0.81 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0041 | 0.0769 | 🔴-0.0729 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 137 | 0.4196 | 0.2482 | 🔴+0.1714 |
| 0.50+ | 143 | 0.5402 | 0.3916 | 🔴+0.1486 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 18 | 0.755 |
| win | <5.0 | ✅learned | 37 | 0.806 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-23T13:00:02.063033+09:00_